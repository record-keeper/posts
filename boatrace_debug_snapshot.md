# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-17T18:10:01.633272+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×72 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×4 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×6  [2026-05-17T18:07:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×3  [2026-05-17T18:07:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×3  [2026-05-17T18:07:06]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×4  [2026-05-17T18:06:40]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-17T17:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-17T17:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×59  [2026-05-17T17:11:24]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×4  [2026-05-17T14:18:06]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×35  [2026-05-17T12:01:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

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


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.88MB / last modified 2026-05-17T18:09:31.844032+09:00

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
p/owpc/pc/race/racelist?rno=7&jcd=07&hd=20260517: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-05-17 18:08:40,603 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=07&hd=20260517: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-05-17 18:08:40,604 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=07&hd=20260517
2026-05-17 18:08:40,604 [ERROR] scraper: racelist fetch failed: jcd=07 rno=7
2026-05-17 18:08:40,604 [WARNING] run_cycle: fetch None: 07/7
2026-05-17 18:08:40,604 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-17 18:09:05,229 [INFO] run_cycle: === run_cycle 18:09:05 ===
2026-05-17 18:09:05,229 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-17 18:09:05,229 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-17 18:09:05,274 [INFO] predictor: Models loaded OK
2026-05-17 18:09:16,335 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=19&hd=20260517: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-05-17 18:09:28,187 [INFO] scraper: odds3t: 120/120 parsed
2026-05-17 18:09:29,343 [INFO] scraper: odds3f: 20/20 parsed
2026-05-17 18:09:30,448 [INFO] scraper: odds2t: 28/30 parsed
2026-05-17 18:09:30,449 [INFO] scraper: odds2f: 14/15 parsed
2026-05-17 18:09:31,563 [INFO] scraper: odds_win: 3/6 parsed
2026-05-17 18:09:31,563 [INFO] scraper: fetch_race 19/7: boats=6 odds=185/191
2026-05-17 18:09:31,576 [INFO] predictor: CALIBRATION_MODE=on
2026-05-17 18:09:31,576 [INFO] predictor: combos: {'win': 3, '2t': 28, '3t': 120}
2026-05-17 18:09:31,584 [INFO] run_cycle: fetched 19/7 [scan]: 151 combos
2026-05-17 18:09:31,778 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 39
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 39
  }
]
```

## Phase別通知記録 (24h)
{'final': 15, 'result': 11, 'scan': 13}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 73
  FINAL_MISSING: 72
  KS_ODDS_DRIFT: 36
  CIRCUIT_BREAKER_NO_ACTION: 25
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 10
  ANOMALY_SCAN_FINAL_RATIO: 7
  CIRCUIT_BREAKER_TRIP: 4
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 12 | 12,900 | 11,100 | -1,800 | 0.86 |
| S01_NAKAANA1 | 37 | 13 | 7,400 | 5,100 | -2,300 | 0.689 |
| S02_TETSUBAN | 24 | 12 | 4,800 | 4,700 | -100 | 0.979 |

## 直近アラート (24h・新しい順)
```
[18:09:31] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 722}
[18:08:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 713}
[18:07:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[18:07:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[18:07:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 712}
[18:06:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 717}
[17:57:06] FINAL_MISSING: {"deadline": "2026-05-17T16:26:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051706111626", "sid": "S00"}
[17:52:06] FINAL_MISSING: {"deadline": "2026-05-17T11:19:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051710071119", "sid": "S00"}
[17:52:06] FINAL_MISSING: {"deadline": "2026-05-17T13:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051706051321", "sid": "S00"}
[17:48:21] FINAL_MISSING: {"deadline": "2026-05-17T12:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051702041214", "sid": "S00"}
```

## 本日残レース: 28件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 120件 登録 / 92件 締切済
- 通知発射: scan=13 nid / final=14 nid / result=10 nid
- predictions: 10 / うち結果DB記録済: 10
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 155R | win | 1 | 0.2290 | 11.6 | 2.66 | 300 | scan=- drift=- | 17:34:32 |
| S01_NAKAANA1 | 154R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=- drift=- | 17:11:21 |
| S00 | 153R | win | 1 | 0.5735 | 27.0 | 15.48 | 300 | scan=- drift=- | 16:34:20 |
| S00 | 152R | win | 1 | 0.4111 | 7.6 | 3.12 | 300 | scan=6.6 drift=+15.2% | 16:07:23 |
| S01_NAKAANA1 | 067R | win | 1 | 0.5735 | 4.7 | 2.70 | 200 | scan=3.4 drift=+38.2% | 14:22:21 |
| S02_TETSUBAN | 218R | win | 1 | 0.4989 | 2.4 | 1.20 | 200 | scan=2.1 drift=+14.3% | 14:16:32 |
| S02_TETSUBAN | 215R | win | 1 | 0.4989 | 2.2 | 1.10 | 200 | scan=2.2 drift=+0.0% | 12:37:20 |
| S00 | 063R | win | 1 | 0.5040 | 4.1 | 2.07 | 300 | scan=- drift=- | 12:27:21 |
| S01_NAKAANA1 | 106R | win | 1 | 0.3177 | 3.3 | 1.05 | 200 | scan=- drift=- | 10:42:21 |
| S01_NAKAANA1 | 105R | win | 1 | 0.5123 | 4.1 | 2.10 | 200 | scan=3.1 drift=+32.3% | 10:15:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 67 | +5.5% | -76.3% | +522.0% | 24 | 11 | 43 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 460.3s |
| **Latency** (scan→final max) | 606.6s |
| **Traffic** (notifications 24h) | 39 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 266 | 0.4525 | 0.2970 | +0.1555 | 🟡+34% | 0.2315 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 193 | 0.4358 | 0.2642 | 0.2276 | 🔴-0.17 | 0.869 |
| S01_NAKAANA1 | win | 44 | 0.4911 | 0.3409 | 0.2348 | 🔴-0.04 | 0.73 |
| S02_TETSUBAN | win | 29 | 0.5045 | 0.4483 | 0.2525 | 🔴-0.02 | 0.862 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 14 | 0.0049 | 0.0714 | 🔴-0.0665 |
| 0.15-0.20 | 7 | 0.1907 | 0.1429 | ✅+0.0479 |
| 0.20-0.30 | 11 | 0.2239 | 0.3636 | 🔴-0.1397 |
| 0.30-0.50 | 121 | 0.4252 | 0.2479 | 🔴+0.1772 |
| 0.50+ | 119 | 0.5408 | 0.3613 | 🔴+0.1794 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 13 | 0.8 |
| win | <5.0 | ✅learned | 29 | 0.715 |
| win | <10.0 | ✅learned | 26 | 0.556 |
| win | <20.0 | ✅learned | 11 | 0.193 |
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
_auto-generated by claude_snapshot.py at 2026-05-17T18:10:01.633272+09:00_