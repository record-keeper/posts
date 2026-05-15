# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-15T17:40:01.551248+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×29 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×63 (24h)
- 🔴 PSI_DRIFT_DETECTED×29 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×10  [2026-05-15T17:30:40]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×33  [2026-05-15T17:07:22]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×33  [2026-05-15T17:07:22]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×33  [2026-05-15T17:07:22]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-05-15T16:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×22  [2026-05-15T15:19:06]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×53  [2026-05-15T13:27:32]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-05-15T11:24:40]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-15T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=13 pred=0.0030 actual=0.0769 gap=-0.0739`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-15T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1907 actual=0.1429 gap=+0.0479`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-15T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2234 actual=0.3000 gap=-0.0766`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-15T06:00:19]
- key: `ROI_STAT|S00: n=183 hit%=25.7% hit_CI[Bonf]=[17.6,35.9]% ROI=0.86 ROI_boot95=[0.62,1.12]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-15T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=183<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-15T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=35 hit%=40.0% hit_CI[Bonf]=[20.4,63.5]% ROI=0.80 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-15T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=35<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-15T06:00:19]
- key: `ORPHAN_SCAN|220 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-15T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=41 hit%=22.0% ROI=0.60 (コスト 12,100/回収 7,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-15T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=31 hit%=32.3% ROI=1.48 (コスト 7,500/回収 11,070)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-15T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=49 hit%=30.6% ROI=1.03 (コスト 12,400/回収 12,720)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-15T06:00:19]
- key: `DRIFT_BUCKET|drift ≥+30%: n=33 hit%=21.2% ROI=0.60 (コスト 8,800/回収 5,280)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.78MB / last modified 2026-05-15T17:39:22.544225+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
d
2026-05-15 17:38:32,629 [INFO] scraper: fetch_race 20/1: boats=6 odds=187/191
2026-05-15 17:38:32,642 [INFO] predictor: CALIBRATION_MODE=on
2026-05-15 17:38:32,642 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-05-15 17:38:32,708 [INFO] run_cycle: fetched 20/1 [final]: 154 combos
2026-05-15 17:38:36,290 [INFO] scraper: odds3t: 120/120 parsed
2026-05-15 17:38:37,480 [INFO] scraper: odds3f: 20/20 parsed
2026-05-15 17:38:38,584 [INFO] scraper: odds2t: 30/30 parsed
2026-05-15 17:38:38,585 [INFO] scraper: odds2f: 15/15 parsed
2026-05-15 17:38:39,896 [INFO] scraper: odds_win: 6/6 parsed
2026-05-15 17:38:39,896 [INFO] scraper: fetch_race 04/12: boats=6 odds=191/191
2026-05-15 17:38:39,909 [INFO] predictor: CALIBRATION_MODE=on
2026-05-15 17:38:39,911 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-15 17:38:39,917 [INFO] run_cycle: fetched 04/12 [scan]: 156 combos
2026-05-15 17:38:40,079 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-15 17:39:05,683 [INFO] run_cycle: === run_cycle 17:39:05 ===
2026-05-15 17:39:05,683 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-15 17:39:05,683 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-15 17:39:05,772 [INFO] predictor: Models loaded OK
2026-05-15 17:39:18,296 [INFO] scraper: odds3t: 120/120 parsed
2026-05-15 17:39:19,453 [INFO] scraper: odds3f: 20/20 parsed
2026-05-15 17:39:20,539 [INFO] scraper: odds2t: 30/30 parsed
2026-05-15 17:39:20,540 [INFO] scraper: odds2f: 13/15 parsed
2026-05-15 17:39:21,619 [INFO] scraper: odds_win: 4/6 parsed
2026-05-15 17:39:21,619 [INFO] scraper: fetch_race 20/1: boats=6 odds=187/191
2026-05-15 17:39:21,632 [INFO] predictor: CALIBRATION_MODE=on
2026-05-15 17:39:21,633 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-05-15 17:39:21,641 [INFO] run_cycle: fetched 20/1 [final]: 154 combos
2026-05-15 17:39:21,932 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 60
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 60
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 13, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 106
  FINAL_MISSING: 63
  KS_ODDS_DRIFT: 29
  PSI_DRIFT_DETECTED: 29
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_NO_ACTION: 5
  ANOMALY_SCAN_FINAL_RATIO: 4
  CIRCUIT_BREAKER_TRIP: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 48 | 12 | 14,400 | 10,620 | -3,780 | 0.738 |
| S01_NAKAANA1 | 37 | 14 | 7,400 | 5,620 | -1,780 | 0.759 |
| S02_TETSUBAN | 27 | 13 | 5,400 | 5,000 | -400 | 0.926 |
| S04_SELL_3T | 12 | 1 | 1,200 | 740 | -460 | 0.617 |

## 直近アラート (24h・新しい順)
```
[17:30:40] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[17:04:29] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[17:04:29] FINAL_MISSING: {"deadline": "2026-05-15T10:30:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051510051030", "sid": "S00"}
[16:56:46] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.556}
[16:56:46] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 139, "n_recent": 112, "psi": 0.421}
[16:45:08] FINAL_MISSING: {"deadline": "2026-05-15T09:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051510020910", "sid": "S00"}
[16:29:22] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[16:04:28] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[16:04:28] FINAL_MISSING: {"deadline": "2026-05-15T10:30:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051510051030", "sid": "S00"}
[15:55:43] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.556}
```

## 本日残レース: 34件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 122件 締切済
- 通知発射: scan=17 nid / final=17 nid / result=9 nid
- predictions: 9 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 047R | win | 1 | 0.5735 | 4.1 | 2.35 | 300 | scan=9.3 drift=-55.9% | 14:55:24 |
| S02_TETSUBAN | 038R | win | 1 | 0.4111 | 2.7 | 1.11 | 200 | scan=- drift=- | 14:09:23 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.8 drift=-7.9% | 12:57:22 |
| S02_TETSUBAN | 215R | win | 1 | 0.4111 | 2.4 | 0.99 | 200 | scan=- drift=- | 12:39:46 |
| S01_NAKAANA1 | 108R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=4.1 drift=-17.1% | 11:56:21 |
| S00 | 134R | win | 1 | 0.4111 | 9.5 | 3.91 | 300 | scan=- drift=- | 11:54:21 |
| S02_TETSUBAN | 213R | win | 1 | 0.4111 | 2.0 | 0.82 | 200 | scan=- drift=- | 11:37:22 |
| S00 | 133R | win | 1 | 0.1371 | 5.5 | 0.75 | 300 | scan=23.2 drift=-76.3% | 11:29:20 |
| S00 | 131R | win | 1 | 0.4111 | 9.7 | 3.99 | 300 | scan=12.7 drift=-23.6% | 10:34:33 |
| S02_TETSUBAN | 0711R | win | 1 | 0.5990 | 2.2 | 1.32 | 200 | scan=2.2 drift=+0.0% | 20:08:46 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 3t | 12 | +11.6% | -41.4% | +75.7% | 5 | 1 | 9 |
| win | 72 | +0.3% | -76.3% | +522.0% | 30 | 16 | 46 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 453.2s |
| **Latency** (scan→final max) | 606.9s |
| **Traffic** (notifications 24h) | 60 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 251 | 0.4525 | 0.2988 | +0.1537 | 🟡+34% | 0.2303 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 187 | 0.4371 | 0.2567 | 0.2263 | 🔴-0.19 | 0.849 |
| S01_NAKAANA1 | win | 37 | 0.4923 | 0.3784 | 0.2341 | 🔴+0.00 | 0.759 |
| S02_TETSUBAN | win | 27 | 0.5049 | 0.4815 | 0.2528 | 🔴-0.01 | 0.926 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0030 | 0.0769 | 🔴-0.0739 |
| 0.15-0.20 | 7 | 0.1907 | 0.1429 | ✅+0.0479 |
| 0.20-0.30 | 10 | 0.2234 | 0.3000 | 🔴-0.0766 |
| 0.30-0.50 | 117 | 0.4250 | 0.2564 | 🔴+0.1686 |
| 0.50+ | 110 | 0.5413 | 0.3636 | 🔴+0.1777 |

## Settlement Ratio データ品質

- 学習済み: 3バンド / fallback: 14バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 13 | 0.8 |
| win | <5.0 | ✅learned | 28 | 0.706 |
| win | <10.0 | ✅learned | 25 | 0.564 |
| win | <20.0 | ⚠️fallback | 9 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-05-15T17:40:01.551248+09:00_