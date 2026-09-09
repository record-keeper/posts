# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-09T09:00:01.656946+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×25 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×59 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×25 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×60  [2026-09-09T08:00:49]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×60  [2026-09-09T08:00:49]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×60  [2026-09-09T08:00:49]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-09T08:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=189<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-09T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=84 hit%=38.1% hit_CI[Bonf]=[24.5,53.8]% ROI=0.65 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-09T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=5 pred=0.1302 actual=0.0000 gap=+0.1302`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-09T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2264 actual=0.2222 gap=+0.0042`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-09T06:00:14]
- key: `ROI_STAT|S00: n=184 hit%=27.7% hit_CI[Bonf]=[19.3,38.1]% ROI=0.94 ROI_boot95=[0.67,1.24]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=184<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-09T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=189 hit%=23.8% hit_CI[Bonf]=[16.1,33.7]% ROI=0.76 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-09-09T06:00:14]
- key: `ORPHAN_SCAN|203 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-09T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=21.6% ROI=0.64 (コスト 10,400/回収 6,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-09T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=42 hit%=31.0% ROI=0.98 (コスト 9,800/回収 9,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-09T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=98 hit%=26.5% ROI=0.93 (コスト 22,600/回収 20,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-09T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=46 hit%=21.7% ROI=0.46 (コスト 10,000/回収 4,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-09T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=45 hit%=15.6% ROI=0.70 (コスト 12,300/回収 8,610)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-09T06:00:14]
- key: `CALIBRATION_LIVE|bt=win: n=457 pred=0.4721 actual=0.2801 error=+0.1920 (+41%) brier=0.2417 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-09T06:00:14]
- key: `CALIBRATION_LIVE|S00(win): n=184 pred=0.4245 hit=0.2772 cal_err=+0.1473 brier=0.2213 BSS=-0.10 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.71MB / last modified 2026-09-09T09:00:06.262614+09:00

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
00
2026-09-09 08:57:04,643 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-09 08:57:04,703 [INFO] predictor: Models loaded OK
2026-09-09 08:57:17,270 [INFO] scraper: odds3t: 120/120 parsed
2026-09-09 08:57:18,375 [INFO] scraper: odds3f: 20/20 parsed
2026-09-09 08:57:19,484 [INFO] scraper: odds2t: 30/30 parsed
2026-09-09 08:57:19,485 [INFO] scraper: odds2f: 13/15 parsed
2026-09-09 08:57:20,591 [INFO] scraper: odds_win: 5/6 parsed
2026-09-09 08:57:20,591 [INFO] scraper: fetch_race 14/2: boats=6 odds=188/191
2026-09-09 08:57:20,595 [INFO] predictor: CALIBRATION_MODE=on
2026-09-09 08:57:20,595 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-09 08:57:20,599 [INFO] run_cycle: fetched 14/2 [scan]: 155 combos
2026-09-09 08:57:20,959 [INFO] race_id: notif: nid=2026090914020910 sid=S01_NAKAANA1 phase=scan rank=B
2026-09-09 08:57:21,352 [INFO] notifier: Discord notify OK (status=204)
2026-09-09 08:57:23,402 [INFO] notifier: Discord notify OK (status=204)
2026-09-09 08:57:23,442 [INFO] run_cycle: SCAN S01_NAKAANA1 鳴門2R B
2026-09-09 08:57:23,551 [INFO] run_cycle: run_cycle done: 1 notifications
2026-09-09 08:58:04,474 [INFO] run_cycle: === run_cycle 08:58:04 ===
2026-09-09 08:58:04,474 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-09 08:58:04,474 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-09 08:58:04,577 [INFO] predictor: Models loaded OK
2026-09-09 08:58:04,683 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-09 08:59:04,475 [INFO] run_cycle: === run_cycle 08:59:04 ===
2026-09-09 08:59:04,475 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-09 08:59:04,475 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-09 08:59:04,529 [INFO] predictor: Models loaded OK
2026-09-09 08:59:04,663 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 56
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 56
  }
]
```

## Phase別通知記録 (24h)
{'final': 22, 'result': 12, 'scan': 22}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 132
  FINAL_MISSING: 59
  CIRCUIT_BREAKER_TRIP: 25
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 5
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 40 | 11 | 12,000 | 11,700 | -300 | 0.975 |
| S01_NAKAANA1 | 40 | 8 | 8,000 | 5,420 | -2,580 | 0.677 |
| S02_TETSUBAN | 16 | 7 | 3,200 | 2,120 | -1,080 | 0.662 |

## 直近アラート (24h・新しい順)
```
[08:00:48] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:48] CIRCUIT_BREAKER_TRIP: {"cost": 8000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 5420, "roi_7d": 0.677, "sid": "S01_NAKAANA1"}
[08:00:48] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:06] CIRCUIT_BREAKER_TRIP: {"cost": 8000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 5420, "roi_7d": 0.677, "sid": "S01_NAKAANA1"}
[06:00:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:55:04] CIRCUIT_BREAKER_TRIP: {"cost": 8000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 5420, "roi_7d": 0.677, "sid": "S01_NAKAANA1"}
[23:47:04] FINAL_MISSING: {"deadline": "2026-09-08T13:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090814101309", "sid": "S00"}
[23:44:04] FINAL_MISSING: {"deadline": "2026-09-08T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090803031208", "sid": "S00"}
[23:31:05] FINAL_MISSING: {"deadline": "2026-09-08T10:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090816011053", "sid": "S00"}
```

## 本日残レース: 141件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 3件 締切済
- 通知発射: scan=1 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 079R | win | 1 | 0.5735 | 2.0 | 1.15 | 200 | scan=- drift=- | 19:01:43 |
| S01_NAKAANA1 | 019R | win | 1 | 0.3177 | 3.8 | 1.21 | 200 | scan=- drift=- | 18:51:30 |
| S00 | 168R | win | 1 | 0.3830 | 6.0 | 2.30 | 300 | scan=8.2 drift=-26.8% | 14:32:31 |
| S00 | 038R | win | 1 | 0.4111 | 7.1 | 2.92 | 300 | scan=- drift=- | 14:21:18 |
| S00 | 166R | win | 1 | 0.5123 | 9.9 | 5.07 | 300 | scan=4.2 drift=+135.7% | 13:24:19 |
| S00 | 046R | win | 1 | 0.0918 | 4.3 | 0.39 | 300 | scan=- drift=- | 13:19:30 |
| S01_NAKAANA1 | 1410R | win | 1 | 0.5174 | 3.3 | 1.71 | 200 | scan=4.5 drift=-26.7% | 13:06:29 |
| S02_TETSUBAN | 035R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=2.2 drift=-9.1% | 12:59:27 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=- drift=- | 12:55:19 |
| S01_NAKAANA1 | 148R | win | 1 | 0.5719 | 4.4 | 2.52 | 200 | scan=3.1 drift=+41.9% | 12:02:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +7.0% | -75.5% | +137.8% | 17 | 8 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 529.4s |
| **Latency** (scan→final max) | 626.7s |
| **Traffic** (notifications 24h) | 56 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 457 | 0.4721 | 0.2801 | +0.1920 | 🟡+41% | 0.2417 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 184 | 0.4245 | 0.2772 | 0.2213 | 🔴-0.10 | 0.939 |
| S01_NAKAANA1 | win | 189 | 0.4857 | 0.2381 | 0.2510 | 🔴-0.38 | 0.762 |
| S02_TETSUBAN | win | 84 | 0.5457 | 0.3810 | 0.2656 | 🔴-0.13 | 0.652 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 5 | 0.1302 | 0.0000 | 🔴+0.1302 |
| 0.15-0.20 | 9 | 0.1773 | 0.2222 | ✅-0.0449 |
| 0.20-0.30 | 9 | 0.2264 | 0.2222 | ✅+0.0042 |
| 0.30-0.50 | 161 | 0.4020 | 0.2484 | 🔴+0.1535 |
| 0.50+ | 269 | 0.5444 | 0.3086 | 🔴+0.2359 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 133 | 0.772 |
| win | <5.0 | ✅learned | 240 | 0.75 |
| win | <10.0 | ✅learned | 118 | 0.471 |
| win | <20.0 | ✅learned | 31 | 0.231 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-09-09T09:00:01.656946+09:00_