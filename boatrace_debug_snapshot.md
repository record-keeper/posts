# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-17T13:40:05.761003+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×92 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×3 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-17T13:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-17T13:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×23  [2026-05-17T13:17:37]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×74  [2026-05-17T13:03:21]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×37  [2026-05-17T13:03:21]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×37  [2026-05-17T13:03:21]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_BET_VOLUME_DROP  ×35  [2026-05-17T12:01:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CIRCUIT_BREAKER_TRIP  ×33  [2026-05-17T10:15:22]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-17T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1907 actual=0.1429 gap=+0.0479`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-17T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2234 actual=0.3000 gap=-0.0766`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-17T06:00:09]
- key: `DRIFT_BUCKET|drift ≥+30%: n=33 hit%=21.2% ROI=0.60 (コスト 8,800/回収 5,280)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-17T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=20 pred=0.3268 actual=0.1500 gap=+0.1768`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-17T06:00:09]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=27 pred=0.5049 hit=0.4815 cal_err=+0.0234 brier=0.2528 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-17T06:00:09]
- key: `ROI_STAT|S00: n=190 hit%=26.3% hit_CI[Bonf]=[18.2,36.4]% ROI=0.87 ROI_boot95=[0.64,1.12]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-17T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=190<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-17T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=40 hit%=35.0% hit_CI[Bonf]=[17.6,57.6]% ROI=0.70 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-17T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=40<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-17T06:00:09]
- key: `ORPHAN_SCAN|234 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-17T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=44 hit%=25.0% ROI=0.66 (コスト 13,000/回収 8,550)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-17T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=29.4% ROI=1.35 (コスト 8,200/回収 11,070)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.87MB / last modified 2026-05-17T13:39:32.066199+09:00

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
_race 02/7: boats=6 odds=191/191
2026-05-17 13:38:21,846 [INFO] predictor: CALIBRATION_MODE=on
2026-05-17 13:38:21,847 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-17 13:38:21,854 [INFO] run_cycle: fetched 02/7 [scan]: 156 combos
2026-05-17 13:38:22,027 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-17 13:39:05,680 [INFO] run_cycle: === run_cycle 13:39:05 ===
2026-05-17 13:39:05,680 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-17 13:39:05,680 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-17 13:39:05,732 [INFO] predictor: Models loaded OK
2026-05-17 13:39:16,978 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=06&hd=20260517: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-05-17 13:39:28,443 [INFO] scraper: odds3t: 120/120 parsed
2026-05-17 13:39:29,526 [INFO] scraper: odds3f: 20/20 parsed
2026-05-17 13:39:30,607 [INFO] scraper: odds2t: 30/30 parsed
2026-05-17 13:39:30,609 [INFO] scraper: odds2f: 15/15 parsed
2026-05-17 13:39:31,677 [INFO] scraper: odds_win: 4/6 parsed
2026-05-17 13:39:31,677 [INFO] scraper: fetch_race 06/6: boats=6 odds=189/191
2026-05-17 13:39:31,689 [INFO] predictor: CALIBRATION_MODE=on
2026-05-17 13:39:31,689 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-05-17 13:39:31,697 [INFO] run_cycle: fetched 06/6 [scan]: 154 combos
2026-05-17 13:39:31,794 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-17 13:40:07,143 [INFO] run_cycle: === run_cycle 13:40:07 ===
2026-05-17 13:40:07,144 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-17 13:40:07,144 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-17 13:40:07,243 [INFO] predictor: Models loaded OK
2026-05-17 13:40:08,067 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 36
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 36
  }
]
```

## Phase別通知記録 (24h)
{'final': 14, 'result': 6, 'scan': 16}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 92
  ANOMALY_SCRAPER_FAILURE_BURST: 55
  KS_ODDS_DRIFT: 29
  CIRCUIT_BREAKER_NO_ACTION: 21
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 15
  ANOMALY_SCAN_FINAL_RATIO: 7
  CIRCUIT_BREAKER_TRIP: 3
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 12 | 12,600 | 10,620 | -1,980 | 0.843 |
| S01_NAKAANA1 | 37 | 14 | 7,400 | 6,140 | -1,260 | 0.83 |
| S02_TETSUBAN | 27 | 13 | 5,400 | 5,000 | -400 | 0.926 |

## 直近アラート (24h・新しい順)
```
[13:34:35] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.279, "baseline_mean": 0.779, "baseline_stdev": 0.086, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 8, "z_score": -3.26}
[13:28:06] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.535}
[13:17:32] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[13:08:33] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.208, "baseline_mean": 0.779, "baseline_stdev": 0.086, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.571, "today_scan_count": 7, "z_score": -2.42}
[13:06:31] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.55}
[13:03:21] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:03:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:50:23] FINAL_MISSING: {"deadline": "2026-05-17T11:19:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051710071119", "sid": "S00"}
[12:44:05] FINAL_MISSING: {"deadline": "2026-05-17T12:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051702041214", "sid": "S00"}
[12:37:35] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.542}
```

## 本日残レース: 75件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 120件 登録 / 45件 締切済
- 通知発射: scan=8 nid / final=6 nid / result=4 nid
- predictions: 4 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 215R | win | 1 | 0.4989 | 2.2 | 1.10 | 200 | scan=2.2 drift=+0.0% | 12:37:20 |
| S00 | 063R | win | 1 | 0.5040 | 4.1 | 2.07 | 300 | scan=- drift=- | 12:27:21 |
| S01_NAKAANA1 | 106R | win | 1 | 0.3177 | 3.3 | 1.05 | 200 | scan=- drift=- | 10:42:21 |
| S01_NAKAANA1 | 105R | win | 1 | 0.5123 | 4.1 | 2.10 | 200 | scan=3.1 drift=+32.3% | 10:15:21 |
| S00 | 197R | win | 1 | 0.5123 | 9.0 | 4.61 | 300 | scan=- drift=- | 18:18:45 |
| S00 | 176R | win | 1 | 0.5476 | 15.6 | 8.54 | 300 | scan=22.3 drift=-30.0% | 13:34:31 |
| S01_NAKAANA1 | 042R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=4.3 drift=-18.6% | 12:23:20 |
| S00 | 107R | win | 1 | 0.0295 | 26.0 | 0.77 | 300 | scan=- drift=- | 11:15:33 |
| S01_NAKAANA1 | 021R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=- drift=- | 10:45:22 |
| S01_NAKAANA1 | 142R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=3.3 drift=+0.0% | 09:07:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 66 | +4.1% | -76.3% | +522.0% | 25 | 12 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 467.1s |
| **Latency** (scan→final max) | 646.5s |
| **Traffic** (notifications 24h) | 36 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 260 | 0.4521 | 0.3000 | +0.1521 | 🟡+34% | 0.2294 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 190 | 0.4363 | 0.2632 | 0.2254 | 🔴-0.16 | 0.866 |
| S01_NAKAANA1 | win | 42 | 0.4886 | 0.3571 | 0.2319 | 🔴-0.01 | 0.764 |
| S02_TETSUBAN | win | 28 | 0.5047 | 0.4643 | 0.2527 | 🔴-0.02 | 0.893 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 14 | 0.0049 | 0.0714 | 🔴-0.0665 |
| 0.15-0.20 | 7 | 0.1907 | 0.1429 | ✅+0.0479 |
| 0.20-0.30 | 10 | 0.2234 | 0.3000 | 🔴-0.0766 |
| 0.30-0.50 | 119 | 0.4247 | 0.2521 | 🔴+0.1726 |
| 0.50+ | 116 | 0.5404 | 0.3707 | 🔴+0.1697 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 13 | 0.8 |
| win | <5.0 | ✅learned | 29 | 0.715 |
| win | <10.0 | ✅learned | 26 | 0.556 |
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
_auto-generated by claude_snapshot.py at 2026-05-17T13:40:05.761003+09:00_