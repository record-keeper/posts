# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-16T15:40:02.020408+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×64 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×14 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_BET_VOLUME_DROP  ×36  [2026-05-16T15:03:31]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×36  [2026-05-16T15:03:31]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×36  [2026-05-16T15:03:31]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×36  [2026-05-16T15:03:31]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-05-16T14:30:37]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-05-16T14:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×38  [2026-05-16T13:27:51]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×42  [2026-05-16T12:41:02]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×14  [2026-05-16T11:01:21]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-16T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=13 pred=0.0030 actual=0.0769 gap=-0.0739`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-16T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1907 actual=0.1429 gap=+0.0479`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-16T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2234 actual=0.3000 gap=-0.0766`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-16T06:00:09]
- key: `DRIFT_BUCKET|drift ≥+30%: n=33 hit%=21.2% ROI=0.60 (コスト 8,800/回収 5,280)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-16T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=20 pred=0.3268 actual=0.1500 gap=+0.1768`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-16T06:00:09]
- key: `ROI_STAT|S00: n=187 hit%=25.7% hit_CI[Bonf]=[17.6,35.8]% ROI=0.85 ROI_boot95=[0.62,1.10]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-16T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=187<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-16T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=37 hit%=37.8% hit_CI[Bonf]=[19.2,61.0]% ROI=0.76 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-16T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=37<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-16T06:00:09]
- key: `ORPHAN_SCAN|225 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-16T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=43 hit%=23.3% ROI=0.61 (コスト 12,700/回収 7,740)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.83MB / last modified 2026-05-16T15:39:18.124325+09:00

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
ds3t: 120/120 parsed
2026-05-16 15:37:44,765 [INFO] scraper: odds3f: 20/20 parsed
2026-05-16 15:37:45,861 [INFO] scraper: odds2t: 30/30 parsed
2026-05-16 15:37:45,862 [INFO] scraper: odds2f: 15/15 parsed
2026-05-16 15:37:46,981 [INFO] scraper: odds_win: 6/6 parsed
2026-05-16 15:37:46,981 [INFO] scraper: fetch_race 03/11: boats=6 odds=191/191
2026-05-16 15:37:46,994 [INFO] predictor: CALIBRATION_MODE=on
2026-05-16 15:37:46,994 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-16 15:37:47,002 [INFO] run_cycle: fetched 03/11 [scan]: 156 combos
2026-05-16 15:37:47,155 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-16 15:38:05,575 [INFO] run_cycle: === run_cycle 15:38:05 ===
2026-05-16 15:38:05,575 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-16 15:38:05,575 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-16 15:38:05,621 [INFO] predictor: Models loaded OK
2026-05-16 15:38:16,682 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=11&jcd=13&hd=20260516: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-05-16 15:38:27,031 [WARNING] scraper: beforeinfo parse failed: jcd=13 rno=11
2026-05-16 15:38:27,032 [WARNING] run_cycle: fetch None: 13/11
2026-05-16 15:38:27,115 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-16 15:39:06,004 [INFO] run_cycle: === run_cycle 15:39:06 ===
2026-05-16 15:39:06,004 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-16 15:39:06,004 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-16 15:39:06,046 [INFO] predictor: Models loaded OK
2026-05-16 15:39:17,390 [WARNING] scraper: beforeinfo parse failed: jcd=13 rno=11
2026-05-16 15:39:17,390 [WARNING] run_cycle: fetch None: 13/11
2026-05-16 15:39:17,485 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 48
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 48
  }
]
```

## Phase別通知記録 (24h)
{'final': 17, 'result': 5, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 134
  FINAL_MISSING: 64
  KS_ODDS_DRIFT: 22
  ANOMALY_SCAN_FINAL_RATIO: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 14
  ANOMALY_BET_VOLUME_DROP: 5
  CIRCUIT_BREAKER_TRIP: 2
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 12 | 14,100 | 10,500 | -3,600 | 0.745 |
| S01_NAKAANA1 | 40 | 14 | 8,000 | 5,620 | -2,380 | 0.703 |
| S02_TETSUBAN | 27 | 13 | 5,400 | 5,000 | -400 | 0.926 |

## 直近アラート (24h・新しい順)
```
[15:39:17] FINAL_MISSING: {"deadline": "2026-05-16T13:07:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051614101307", "sid": "S00"}
[15:32:31] FINAL_MISSING: {"deadline": "2026-05-16T10:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051614061059", "sid": "S00"}
[15:25:32] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.557}
[15:21:35] FINAL_MISSING: {"deadline": "2026-05-16T11:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051610081150", "sid": "S00"}
[15:14:59] FINAL_MISSING: {"deadline": "2026-05-16T12:43:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051603051243", "sid": "S01_NAKAANA1"}
[15:14:59] FINAL_MISSING: {"deadline": "2026-05-16T12:43:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051603051243", "sid": "S00"}
[15:03:31] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:03:31] FINAL_MISSING: {"deadline": "2026-05-16T11:32:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051617021132", "sid": "S00"}
[15:03:31] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[15:00:20] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 13.3, "baseline_n_days": 7, "baseline_stdev": 3.3, "hour": 15, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 5, "z_score": -2.51}
```

## 本日残レース: 62件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 94件 締切済
- 通知発射: scan=20 nid / final=15 nid / result=5 nid
- predictions: 5 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 8件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 176R | win | 1 | 0.5476 | 15.6 | 8.54 | 300 | scan=22.3 drift=-30.0% | 13:34:31 |
| S01_NAKAANA1 | 042R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=4.3 drift=-18.6% | 12:23:20 |
| S00 | 107R | win | 1 | 0.0295 | 26.0 | 0.77 | 300 | scan=- drift=- | 11:15:33 |
| S01_NAKAANA1 | 021R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=- drift=- | 10:45:22 |
| S01_NAKAANA1 | 142R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=3.3 drift=+0.0% | 09:07:20 |
| S00 | 047R | win | 1 | 0.5735 | 4.1 | 2.35 | 300 | scan=9.3 drift=-55.9% | 14:55:24 |
| S02_TETSUBAN | 038R | win | 1 | 0.4111 | 2.7 | 1.11 | 200 | scan=- drift=- | 14:09:23 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.8 drift=-7.9% | 12:57:22 |
| S02_TETSUBAN | 215R | win | 1 | 0.4111 | 2.4 | 0.99 | 200 | scan=- drift=- | 12:39:46 |
| S01_NAKAANA1 | 108R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=4.1 drift=-17.1% | 11:56:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 72 | +2.0% | -76.3% | +522.0% | 29 | 14 | 45 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 477.7s |
| **Latency** (scan→final max) | 646.5s |
| **Traffic** (notifications 24h) | 48 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 256 | 0.4517 | 0.2969 | +0.1548 | 🟡+34% | 0.2295 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 189 | 0.4355 | 0.2593 | 0.2250 | 🔴-0.17 | 0.854 |
| S01_NAKAANA1 | win | 40 | 0.4923 | 0.3500 | 0.2350 | 🔴-0.03 | 0.703 |
| S02_TETSUBAN | win | 27 | 0.5049 | 0.4815 | 0.2528 | 🔴-0.01 | 0.926 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 14 | 0.0049 | 0.0714 | 🔴-0.0665 |
| 0.15-0.20 | 7 | 0.1907 | 0.1429 | ✅+0.0479 |
| 0.20-0.30 | 10 | 0.2234 | 0.3000 | 🔴-0.0766 |
| 0.30-0.50 | 118 | 0.4249 | 0.2542 | 🔴+0.1707 |
| 0.50+ | 113 | 0.5413 | 0.3628 | 🔴+0.1784 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 13 | 0.8 |
| win | <5.0 | ✅learned | 28 | 0.706 |
| win | <10.0 | ✅learned | 25 | 0.564 |
| win | <20.0 | ✅learned | 10 | 0.185 |
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
_auto-generated by claude_snapshot.py at 2026-05-16T15:40:02.020408+09:00_